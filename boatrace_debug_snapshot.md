# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-08-13T14:50:01.666425+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×43 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×144 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×43 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-13T14:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-08-13T14:30:02]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×45  [2026-08-13T14:05:19]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 CIRCUIT_BREAKER_TRIP  ×94  [2026-08-13T14:03:32]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×94  [2026-08-13T14:03:32]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×47  [2026-08-13T14:03:32]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×59  [2026-08-13T11:33:40]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_BET_VOLUME_DROP  ×45  [2026-08-13T10:00:24]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-13T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S00: n=165<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-13T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=69<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-08-13T06:00:10]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=166<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-08-13T06:00:10]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=11 pred=0.1216 actual=0.1818 gap=-0.0602`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-13T06:00:10]
- key: `ROI_STAT|S00: n=165 hit%=21.8% hit_CI[Bonf]=[14.0,32.3]% ROI=0.62 ROI_boot95=[0.41,0.85]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-13T06:00:10]
- key: `ROI_STAT|S01_NAKAANA1: n=166 hit%=21.7% hit_CI[Bonf]=[13.9,32.2]% ROI=0.67 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-08-13T06:00:10]
- key: `ROI_STAT|S02_TETSUBAN: n=69 hit%=55.1% hit_CI[Bonf]=[38.2,70.9]% ROI=0.92 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-08-13T06:00:10]
- key: `ORPHAN_SCAN|178 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-13T06:00:10]
- key: `DRIFT_BUCKET|drift ≤-30%: n=38 hit%=21.1% ROI=0.62 (コスト 10,900/回収 6,770)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-13T06:00:10]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=35 hit%=31.4% ROI=0.79 (コスト 8,600/回収 6,810)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-13T06:00:10]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=67 hit%=26.9% ROI=0.58 (コスト 15,600/回収 8,990)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-08-13T06:00:10]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=46 hit%=26.1% ROI=0.53 (コスト 10,600/回収 5,620)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 10.29MB / last modified 2026-08-13T14:49:34.709971+09:00

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
8,964 [INFO] scraper: odds2f: 15/15 parsed
2026-08-13 14:49:20,053 [INFO] scraper: odds_win: 3/6 parsed
2026-08-13 14:49:20,053 [INFO] scraper: fetch_race 03/9: boats=6 odds=188/191
2026-08-13 14:49:20,056 [INFO] predictor: CALIBRATION_MODE=on
2026-08-13 14:49:20,057 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-08-13 14:49:20,060 [INFO] run_cycle: fetched 03/9 [final]: 153 combos
2026-08-13 14:49:20,194 [INFO] race_id: notif: nid=2026081303091452 sid=S02_TETSUBAN phase=final rank=B
2026-08-13 14:49:20,587 [INFO] notifier: Discord notify OK (status=204)
2026-08-13 14:49:20,914 [INFO] notifier: Discord notify OK (status=204)
2026-08-13 14:49:20,933 [INFO] run_cycle: FINAL S02_TETSUBAN 江戸川9R B
2026-08-13 14:49:24,414 [INFO] scraper: odds3t: 120/120 parsed
2026-08-13 14:49:25,505 [INFO] scraper: odds3f: 20/20 parsed
2026-08-13 14:49:26,613 [INFO] scraper: odds2t: 30/30 parsed
2026-08-13 14:49:26,614 [INFO] scraper: odds2f: 15/15 parsed
2026-08-13 14:49:27,680 [INFO] scraper: odds_win: 6/6 parsed
2026-08-13 14:49:27,680 [INFO] scraper: fetch_race 04/7: boats=6 odds=191/191
2026-08-13 14:49:27,683 [INFO] predictor: CALIBRATION_MODE=on
2026-08-13 14:49:27,683 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-08-13 14:49:27,687 [INFO] run_cycle: fetched 04/7 [scan]: 156 combos
2026-08-13 14:49:31,166 [INFO] scraper: odds3t: 120/120 parsed
2026-08-13 14:49:32,273 [INFO] scraper: odds3f: 20/20 parsed
2026-08-13 14:49:33,387 [INFO] scraper: odds2t: 29/30 parsed
2026-08-13 14:49:33,388 [INFO] scraper: odds2f: 14/15 parsed
2026-08-13 14:49:34,465 [INFO] scraper: odds_win: 3/6 parsed
2026-08-13 14:49:34,465 [INFO] scraper: fetch_race 08/10: boats=6 odds=186/191
2026-08-13 14:49:34,468 [INFO] predictor: CALIBRATION_MODE=on
2026-08-13 14:49:34,468 [INFO] predictor: combos: {'win': 3, '2t': 29, '3t': 120}
2026-08-13 14:49:34,473 [INFO] run_cycle: fetched 08/10 [scan]: 152 combos
2026-08-13 14:49:34,612 [INFO] run_cycle: run_cycle done: 1 notifications

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
    "c": 92
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 92
  }
]
```

## Phase別通知記録 (24h)
{'final': 33, 'result': 13, 'scan': 46}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 173
  FINAL_MISSING: 144
  ANOMALY_SCAN_FINAL_RATIO: 68
  CIRCUIT_BREAKER_TRIP: 43
  CIRCUIT_BREAKER_NO_ACTION: 34
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 37 | 8 | 11,100 | 6,390 | -4,710 | 0.576 |
| S01_NAKAANA1 | 48 | 8 | 9,600 | 4,940 | -4,660 | 0.515 |
| S02_TETSUBAN | 21 | 12 | 4,200 | 3,620 | -580 | 0.862 |

## 直近アラート (24h・新しい順)
```
[14:48:39] FINAL_MISSING: {"deadline": "2026-08-13T11:16:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081302021116", "sid": "S00"}
[14:45:52] ANOMALY_SCAN_FINAL_RATIO: {"abs_drop": 0.238, "baseline_mean": 0.784, "baseline_stdev": 0.096, "kind": "ANOMALY_SCAN_FINAL_RATIO", "today_ratio": 0.545, "today_scan_count": 22, "z_score": -2.47}
[14:38:25] FINAL_MISSING: {"deadline": "2026-08-13T14:08:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081306061408", "sid": "S00"}
[14:35:26] CIRCUIT_BREAKER_TRIP: {"cost": 9600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 48, "payout": 4940, "roi_7d": 0.515, "sid": "S01_NAKAANA1"}
[14:35:26] FINAL_MISSING: {"deadline": "2026-08-13T10:02:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081323041002", "sid": "S00"}
[14:30:42] FINAL_MISSING: {"deadline": "2026-08-13T11:59:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081306021159", "sid": "S00"}
[14:25:04] FINAL_MISSING: {"deadline": "2026-08-13T13:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081304051355", "sid": "S00"}
[14:23:19] FINAL_MISSING: {"deadline": "2026-08-13T11:52:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081321081152", "sid": "S00"}
[14:17:57] FINAL_MISSING: {"deadline": "2026-08-13T12:47:00+09:00", "kind": "FINAL_MISSING", "nid": "2026081322021247", "sid": "S00"}
[14:13:33] CIRCUIT_BREAKER_TRIP: {"cost": 11100, "kind": "CIRCUIT_BREAKER_TRIP", "n": 37, "payout": 6390, "roi_7d": 0.576, "sid": "S00"}
```

## 本日残レース: 94件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 180件 登録 / 86件 締切済
- 通知発射: scan=22 nid / final=16 nid / result=7 nid
- predictions: 8 / うち結果DB記録済: 7
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 9件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 039R | win | 1 | 0.5891 | 2.3 | 1.35 | 200 | scan=- drift=- | 14:49:20 |
| S00 | 037R | win | 1 | 0.1957 | 5.7 | 1.12 | 300 | scan=5.5 drift=+3.6% | 13:53:27 |
| S00 | 224R | win | 1 | 0.3177 | 5.2 | 1.65 | 300 | scan=- drift=- | 13:40:20 |
| S01_NAKAANA1 | 087R | win | 1 | 0.4989 | 3.7 | 1.85 | 200 | scan=3.4 drift=+8.8% | 13:34:30 |
| S01_NAKAANA1 | 065R | win | 1 | 0.5014 | 3.0 | 1.50 | 200 | scan=4.0 drift=-25.0% | 13:30:20 |
| S01_NAKAANA1 | 024R | win | 1 | 0.4989 | 3.1 | 1.55 | 200 | scan=3.0 drift=+3.3% | 12:11:18 |
| S00 | 163R | win | 1 | 0.3177 | 4.0 | 1.27 | 300 | scan=- drift=- | 11:36:19 |
| S00 | 021R | win | 1 | 0.5123 | 4.0 | 2.05 | 300 | scan=- drift=- | 10:45:30 |
| S01_NAKAANA1 | 196R | win | 1 | 0.5400 | 4.3 | 2.32 | 200 | scan=4.2 drift=+2.4% | 19:53:30 |
| S00 | 194R | win | 1 | 0.5735 | 5.3 | 3.04 | 300 | scan=10.9 drift=-51.4% | 19:00:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 66 | +8.5% | -53.3% | +287.7% | 19 | 7 | 44 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 482.3s |
| **Latency** (scan→final max) | 637.6s |
| **Traffic** (notifications 24h) | 92 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,200円 used |
| **Saturation** (S01_NAKAANA1) | 600円 used |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 402 | 0.4696 | 0.2761 | +0.1934 | 🟡+41% | 0.2381 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 167 | 0.4233 | 0.2216 | 0.2282 | 🔴-0.32 | 0.616 |
| S01_NAKAANA1 | win | 167 | 0.4919 | 0.2156 | 0.2478 | 🔴-0.47 | 0.665 |
| S02_TETSUBAN | win | 68 | 0.5281 | 0.5588 | 0.2387 | ✅+0.03 | 0.937 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 10 | 0.1201 | 0.2000 | 🔴-0.0799 |
| 0.15-0.20 | 10 | 0.1863 | 0.1000 | 🔴+0.0863 |
| 0.20-0.30 | 8 | 0.2235 | 0.3750 | 🔴-0.1515 |
| 0.30-0.50 | 154 | 0.4211 | 0.2273 | 🔴+0.1938 |
| 0.50+ | 219 | 0.5432 | 0.3196 | 🔴+0.2236 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 108 | 0.771 |
| win | <5.0 | ✅learned | 182 | 0.724 |
| win | <10.0 | ✅learned | 92 | 0.449 |
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
_auto-generated by claude_snapshot.py at 2026-08-13T14:50:01.666425+09:00_