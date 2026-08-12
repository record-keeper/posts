# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-12T15:50:01.846043+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×26 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×54 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×26 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-12T15:30:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×44  [2026-08-12T15:06:45]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×92  [2026-08-12T15:04:28]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×92  [2026-08-12T15:04:28]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×46  [2026-08-12T15:04:28]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-12T15:00:06]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×20  [2026-08-12T12:58:06]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-12T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=69<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-08-12T06:00:16]
- key: `ORPHAN_SCAN|170 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-12T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=167<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-12T06:00:16]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=11 pred=0.1216 actual=0.1818 gap=-0.0602`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-12T06:00:16]
- key: `ROI_STAT|S00: n=162 hit%=22.2% hit_CI[Bonf]=[14.3,32.9]% ROI=0.63 ROI_boot95=[0.42,0.87]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-12T06:00:16]
- key: `INSUFFICIENT_SAMPLE|S00: n=162<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-12T06:00:16]
- key: `ROI_STAT|S01_NAKAANA1: n=167 hit%=22.2% hit_CI[Bonf]=[14.3,32.6]% ROI=0.68 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-12T06:00:16]
- key: `ROI_STAT|S02_TETSUBAN: n=69 hit%=52.2% hit_CI[Bonf]=[35.5,68.3]% ROI=0.89 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-12T06:00:16]
- key: `DRIFT_BUCKET|drift ≤-30%: n=37 hit%=21.6% ROI=0.64 (コスト 10,600/回収 6,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-12T06:00:16]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=34 hit%=32.4% ROI=0.82 (コスト 8,300/回収 6,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-12T06:00:16]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=68 hit%=26.5% ROI=0.57 (コスト 15,800/回収 8,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-12T06:00:16]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=47 hit%=23.4% ROI=0.49 (コスト 10,900/回収 5,340)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-12T06:00:16]
- key: `DRIFT_BUCKET|drift ≥+30%: n=36 hit%=25.0% ROI=0.97 (コスト 9,900/回収 9,620)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 10.17MB / last modified 2026-08-12T15:49:33.906052+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
rust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-12 15:49:03,673 [INFO] predictor: Models loaded OK
2026-08-12 15:49:16,403 [INFO] scraper: odds3t: 120/120 parsed
2026-08-12 15:49:17,511 [INFO] scraper: odds3f: 20/20 parsed
2026-08-12 15:49:18,584 [INFO] scraper: odds2t: 30/30 parsed
2026-08-12 15:49:18,585 [INFO] scraper: odds2f: 15/15 parsed
2026-08-12 15:49:19,719 [INFO] scraper: odds_win: 6/6 parsed
2026-08-12 15:49:19,719 [INFO] scraper: fetch_race 20/2: boats=6 odds=191/191
2026-08-12 15:49:19,723 [INFO] predictor: CALIBRATION_MODE=on
2026-08-12 15:49:19,723 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-12 15:49:19,727 [INFO] run_cycle: fetched 20/2 [final]: 156 combos
2026-08-12 15:49:23,433 [INFO] scraper: odds3t: 120/120 parsed
2026-08-12 15:49:24,551 [INFO] scraper: odds3f: 20/20 parsed
2026-08-12 15:49:25,632 [INFO] scraper: odds2t: 30/30 parsed
2026-08-12 15:49:25,633 [INFO] scraper: odds2f: 15/15 parsed
2026-08-12 15:49:26,749 [INFO] scraper: odds_win: 6/6 parsed
2026-08-12 15:49:26,749 [INFO] scraper: fetch_race 02/11: boats=6 odds=191/191
2026-08-12 15:49:26,751 [INFO] predictor: CALIBRATION_MODE=on
2026-08-12 15:49:26,751 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-12 15:49:26,755 [INFO] run_cycle: fetched 02/11 [scan]: 156 combos
2026-08-12 15:49:30,249 [INFO] scraper: odds3t: 120/120 parsed
2026-08-12 15:49:31,331 [INFO] scraper: odds3f: 20/20 parsed
2026-08-12 15:49:32,407 [INFO] scraper: odds2t: 30/30 parsed
2026-08-12 15:49:32,408 [INFO] scraper: odds2f: 15/15 parsed
2026-08-12 15:49:33,514 [INFO] scraper: odds_win: 5/6 parsed
2026-08-12 15:49:33,514 [INFO] scraper: fetch_race 06/10: boats=6 odds=190/191
2026-08-12 15:49:33,516 [INFO] predictor: CALIBRATION_MODE=on
2026-08-12 15:49:33,516 [INFO] predictor: combos: {'win': 5, '2t': 30, '3t': 120}
2026-08-12 15:49:33,520 [INFO] run_cycle: fetched 06/10 [scan]: 155 combos
2026-08-12 15:49:33,635 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 97
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 97
  }
]
```

## Phase別通知記録 (24h)
{'final': 38, 'result': 16, 'scan': 43}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 85
  FINAL_MISSING: 54
  ANOMALY_SCAN_FINAL_RATIO: 35
  CIRCUIT_BREAKER_NO_ACTION: 27
  CIRCUIT_BREAKER_TRIP: 26
  STRATEGY_CI_FAIL: 17
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 32 | 7 | 9,600 | 6,000 | -3,600 | 0.625 |
| S01_NAKAANA1 | 48 | 9 | 9,600 | 5,300 | -4,300 | 0.552 |
| S02_TETSUBAN | 20 | 11 | 4,000 | 3,340 | -660 | 0.835 |

## 直近アラート (24h・新しい順)
```
[15:45:50] FINAL_MISSING: {"deadline": "2026-08-12T12:14:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081202041214", "sid": "S00"}
[15:40:27] FINAL_MISSING: {"deadline": "2026-08-12T12:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081203031208", "sid": "S00"}
[15:36:28] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.241, "baseline_mean": 0.818, "baseline_stdev": 0.082, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.577, "today_scan_count": 26, "z_score": -2.92}
[15:32:41] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.279, "baseline_mean": 0.818, "baseline_stdev": 0.082, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.538, "today_scan_count": 26, "z_score": -3.39}
[15:29:53] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.258, "baseline_mean": 0.818, "baseline_stdev": 0.082, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.56, "today_scan_count": 25, "z_score": -3.13}
[15:26:32] FINAL_MISSING: {"deadline": "2026-08-12T13:56:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081203071356", "sid": "S00"}
[15:22:44] FINAL_MISSING: {"deadline": "2026-08-12T10:50:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081221061050", "sid": "S00"}
[15:21:21] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.209, "baseline_mean": 0.818, "baseline_stdev": 0.082, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.609, "today_scan_count": 23, "z_score": -2.54}
[15:19:47] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.181, "baseline_mean": 0.818, "baseline_stdev": 0.082, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.636, "today_scan_count": 22, "z_score": -2.2}
[15:16:32] FINAL_MISSING: {"deadline": "2026-08-12T11:45:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081202031145", "sid": "S00"}
```

## 本日残レース: 72件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 108件 締切済
- 通知発射: scan=26 nid / final=19 nid / result=7 nid
- predictions: 9 / うち結果DB記録済: 8
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 11件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 1610R | win | 1 | 0.4111 | 2.5 | 1.03 | 200 | scan=2.1 drift=+19.0% | 15:36:19 |
| S00 | 011R | win | 1 | 0.5123 | 6.5 | 3.33 | 300 | scan=4.5 drift=+44.4% | 15:14:19 |
| S01_NAKAANA1 | 088R | win | 1 | 0.5476 | 4.9 | 2.68 | 200 | scan=4.7 drift=+4.3% | 14:05:20 |
| S02_TETSUBAN | 036R | win | 1 | 0.5891 | 2.3 | 1.35 | 200 | scan=- drift=- | 13:26:29 |
| S00 | 044R | win | 1 | 0.5123 | 7.5 | 3.84 | 300 | scan=9.1 drift=-17.6% | 13:21:19 |
| S01_NAKAANA1 | 223R | win | 1 | 0.5990 | 3.1 | 1.86 | 200 | scan=- drift=- | 13:16:19 |
| S00 | 032R | win | 1 | 0.4980 | 4.0 | 1.99 | 300 | scan=- drift=- | 11:39:18 |
| S01_NAKAANA1 | 032R | win | 1 | 0.4980 | 3.7 | 1.84 | 200 | scan=- drift=- | 11:38:19 |
| S02_TETSUBAN | 211R | win | 1 | 0.5334 | 2.1 | 1.12 | 200 | scan=- drift=- | 08:29:19 |
| S02_TETSUBAN | 079R | win | 1 | 0.4989 | 2.6 | 1.30 | 200 | scan=2.5 drift=+4.0% | 19:08:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 63 | +9.3% | -53.3% | +287.7% | 18 | 7 | 43 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 448.4s |
| **Latency** (scan→final max) | 616.7s |
| **Traffic** (notifications 24h) | 97 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 399 | 0.4694 | 0.2732 | +0.1962 | 🟡+42% | 0.2367 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 164 | 0.4227 | 0.2195 | 0.2262 | 🔴-0.32 | 0.62 |
| S01_NAKAANA1 | win | 166 | 0.4901 | 0.2169 | 0.2461 | 🔴-0.45 | 0.669 |
| S02_TETSUBAN | win | 69 | 0.5305 | 0.5362 | 0.2391 | ✅+0.04 | 0.903 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 11 | 0.1216 | 0.1818 | 🔴-0.0602 |
| 0.15-0.20 | 9 | 0.1852 | 0.1111 | 🔴+0.0741 |
| 0.20-0.30 | 8 | 0.2235 | 0.3750 | 🔴-0.1515 |
| 0.30-0.50 | 153 | 0.4212 | 0.2157 | 🔴+0.2055 |
| 0.50+ | 217 | 0.5435 | 0.3226 | 🔴+0.2210 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 107 | 0.773 |
| win | <5.0 | ✅learned | 182 | 0.724 |
| win | <10.0 | ✅learned | 91 | 0.451 |
| win | <20.0 | ✅learned | 30 | 0.227 |
| win | <50.0 | ⚠️fallback | 6 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-08-12T15:50:01.846043+09:00_