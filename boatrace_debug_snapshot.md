# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-27T13:00:01.699040+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×72 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×9 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-27T13:00:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×14  [2026-08-27T12:53:35]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×23  [2026-08-27T12:37:24]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-08-27T12:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×134  [2026-08-27T12:03:21]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×57  [2026-08-27T12:03:21]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-08-27T12:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×24  [2026-08-27T11:03:42]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_BET_VOLUME_DROP  ×29  [2026-08-27T10:00:30]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-27T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=81<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-27T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=166<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-27T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=10 pred=0.2255 actual=0.3000 gap=-0.0745`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-27T06:00:10]
- key: `DRIFT_BUCKET|drift ≤-30%: n=37 hit%=18.9% ROI=0.60 (コスト 10,700/回収 6,410)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-27T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=10 pred=0.1249 actual=0.1000 gap=+0.0249`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-27T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=35 pred=0.3201 actual=0.3429 gap=-0.0228`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-27T06:00:10]
- key: `ROI_STAT|S00: n=166 hit%=27.1% hit_CI[Bonf]=[18.4,38.0]% ROI=0.86 ROI_boot95=[0.59,1.15]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-27T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=189 hit%=25.9% hit_CI[Bonf]=[17.9,36.0]% ROI=0.83 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-27T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=189<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-08-27T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=81 hit%=42.0% hit_CI[Bonf]=[27.6,57.8]% ROI=0.69 ROI_boot95=[0.5`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-08-27T06:00:10]
- key: `ORPHAN_SCAN|197 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 11.61MB / last modified 2026-08-27T13:00:04.254352+09:00

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
dds2f: 15/15 parsed
2026-08-27 12:58:43,210 [INFO] scraper: odds_win: 3/6 parsed
2026-08-27 12:58:43,210 [INFO] scraper: fetch_race 08/6: boats=6 odds=188/191
2026-08-27 12:58:43,214 [INFO] predictor: CALIBRATION_MODE=on
2026-08-27 12:58:43,214 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-08-27 12:58:43,218 [INFO] run_cycle: fetched 08/6 [final]: 153 combos
2026-08-27 12:58:45,672 [WARNING] scraper: beforeinfo parse failed: jcd=18 rno=10
2026-08-27 12:58:45,672 [WARNING] run_cycle: fetch None: 18/10
2026-08-27 12:58:45,672 [INFO] run_cycle: run_cycle done: 0 notifications
2026-08-27 12:59:04,162 [INFO] run_cycle: === run_cycle 12:59:04 ===
2026-08-27 12:59:04,162 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-08-27 12:59:04,162 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-08-27 12:59:04,193 [INFO] predictor: Models loaded OK
2026-08-27 12:59:15,244 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=6&jcd=08&hd=20260827: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-08-27 12:59:26,852 [INFO] scraper: odds3t: 120/120 parsed
2026-08-27 12:59:27,990 [INFO] scraper: odds3f: 20/20 parsed
2026-08-27 12:59:29,160 [INFO] scraper: odds2t: 30/30 parsed
2026-08-27 12:59:29,161 [INFO] scraper: odds2f: 15/15 parsed
2026-08-27 12:59:30,261 [INFO] scraper: odds_win: 6/6 parsed
2026-08-27 12:59:30,262 [INFO] scraper: fetch_race 08/6: boats=6 odds=191/191
2026-08-27 12:59:30,265 [INFO] predictor: CALIBRATION_MODE=on
2026-08-27 12:59:30,265 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-27 12:59:30,269 [INFO] run_cycle: fetched 08/6 [final]: 156 combos
2026-08-27 12:59:32,585 [WARNING] scraper: beforeinfo parse failed: jcd=18 rno=10
2026-08-27 12:59:32,585 [WARNING] run_cycle: fetch None: 18/10
2026-08-27 12:59:32,586 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 72
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 72
  }
]
```

## Phase別通知記録 (24h)
{'final': 27, 'result': 17, 'scan': 28}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 120
  FINAL_MISSING: 72
  CIRCUIT_BREAKER_NO_ACTION: 20
  ANOMALY_SCAN_FINAL_RATIO: 18
  STRATEGY_CI_FAIL: 17
  CIRCUIT_BREAKER_TRIP: 9
  ANOMALY_BET_VOLUME_SPIKE: 4
  ANOMALY_BET_VOLUME_DROP: 2
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 40 | 9 | 12,000 | 7,560 | -4,440 | 0.63 |
| S01_NAKAANA1 | 51 | 14 | 10,200 | 6,940 | -3,260 | 0.68 |
| S02_TETSUBAN | 16 | 6 | 3,200 | 2,420 | -780 | 0.756 |

## 直近アラート (24h・新しい順)
```
[12:54:29] FINAL_MISSING: {"deadline": "2026-08-27T11:24:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082709031124", "sid": "S00"}
[12:53:35] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[12:52:15] CIRCUIT_BREAKER_TRIP: {"cost": 12000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 40, "payout": 7560, "roi_7d": 0.63, "sid": "S00"}
[12:52:15] FINAL_MISSING: {"deadline": "2026-08-27T10:21:00+09:00", "kind": "FINAL_MISSING", "nid": "2026082714051021", "sid": "S00"}
[12:50:48] CIRCUIT_BREAKER_TRIP: {"cost": 12300, "kind": "CIRCUIT_BREAKER_TRIP", "n": 41, "payout": 8220, "roi_7d": 0.668, "sid": "S00"}
[12:50:48] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.178, "baseline_mean": 0.803, "baseline_stdev": 0.046, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.625, "today_scan_count": 8, "z_score": -3.84}
[12:40:45] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[12:40:45] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.303, "baseline_mean": 0.803, "baseline_stdev": 0.046, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.5, "today_scan_count": 8, "z_score": -6.53}
[12:39:26] CIRCUIT_BREAKER_TRIP: {"cost": 10200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 51, "payout": 6940, "roi_7d": 0.68, "sid": "S01_NAKAANA1"}
[12:37:24] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.231, "baseline_mean": 0.803, "baseline_stdev": 0.046, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.571, "today_scan_count": 7, "z_score": -4.99}
```

## 本日残レース: 96件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 156件 登録 / 60件 締切済
- 通知発射: scan=8 nid / final=7 nid / result=5 nid
- predictions: 7 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 3件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S00 | 096R | win | 1 | 0.4989 | 4.8 | 2.39 | 300 | scan=4.0 drift=+20.0% | 12:50:32 |
| S01_NAKAANA1 | 109R | win | 1 | 0.4111 | 4.7 | 1.93 | 200 | scan=4.9 drift=-4.1% | 12:37:19 |
| S00 | 149R | win | 1 | 0.5735 | 4.5 | 2.58 | 300 | scan=4.0 drift=+12.5% | 12:19:18 |
| S01_NAKAANA1 | 108R | win | 1 | 0.5110 | 3.3 | 1.69 | 200 | scan=- drift=- | 12:04:42 |
| S01_NAKAANA1 | 173R | win | 1 | 0.4957 | 3.0 | 1.49 | 200 | scan=- drift=- | 11:43:18 |
| S01_NAKAANA1 | 146R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=3.7 drift=-5.4% | 10:46:44 |
| S00 | 111R | win | 1 | 0.0918 | 21.7 | 1.99 | 300 | scan=15.7 drift=+38.2% | 10:29:18 |
| S02_TETSUBAN | 2011R | win | 1 | 0.5334 | 2.3 | 1.23 | 200 | scan=- drift=- | 20:05:42 |
| S02_TETSUBAN | 209R | win | 1 | 0.5891 | 2.2 | 1.30 | 200 | scan=2.4 drift=-8.3% | 19:05:31 |
| S01_NAKAANA1 | 154R | win | 1 | 0.4111 | 3.5 | 1.44 | 200 | scan=3.1 drift=+12.9% | 16:32:29 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 58 | +1.9% | -79.6% | +320.7% | 23 | 9 | 45 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 531.0s |
| **Latency** (scan→final max) | 615.9s |
| **Traffic** (notifications 24h) | 72 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 900円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 436 | 0.4704 | 0.2936 | +0.1769 | 🟡+38% | 0.2398 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 168 | 0.4170 | 0.2738 | 0.2206 | 🔴-0.11 | 0.859 |
| S01_NAKAANA1 | win | 190 | 0.4890 | 0.2579 | 0.2491 | 🔴-0.30 | 0.824 |
| S02_TETSUBAN | win | 78 | 0.5404 | 0.4231 | 0.2583 | 🔴-0.06 | 0.701 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 10 | 0.1249 | 0.1000 | ✅+0.0249 |
| 0.15-0.20 | 10 | 0.1815 | 0.2000 | ✅-0.0185 |
| 0.20-0.30 | 10 | 0.2255 | 0.3000 | 🔴-0.0745 |
| 0.30-0.50 | 154 | 0.4114 | 0.2403 | 🔴+0.1712 |
| 0.50+ | 250 | 0.5451 | 0.3400 | 🔴+0.2051 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 120 | 0.775 |
| win | <5.0 | ✅learned | 222 | 0.749 |
| win | <10.0 | ✅learned | 105 | 0.454 |
| win | <20.0 | ✅learned | 30 | 0.227 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-08-27T13:00:01.699040+09:00_