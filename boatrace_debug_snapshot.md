# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-30T05:50:01.849361+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×40 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×52 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×40 (24h)
- 🔴 PSI_DRIFT_DETECTED×28 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-05-30T05:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×2  [2026-05-30T05:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CIRCUIT_BREAKER_TRIP  ×102  [2026-05-29T23:09:05]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×102  [2026-05-29T23:09:05]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×51  [2026-05-29T23:09:05]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×51  [2026-05-29T23:09:05]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×22  [2026-05-29T20:08:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 PSI_DRIFT_DETECTED  ×43  [2026-05-29T15:04:22]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×15  [2026-05-29T14:45:37]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×11  [2026-05-29T12:18:41]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🔴 SEND_WITHOUT_DBREC  ×1  [2026-05-29T12:00:44]
- key: `SEND_WITHOUT_DBREC|`
- **FIX**: record_notification の例外→DB書込エラー原因特定（WAL、ロック）

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-29T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=176<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-29T06:00:11]
- key: `ORPHAN_SCAN|234 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-29T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=26 pred=0.3234 actual=0.2308 gap=+0.0926`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-29T06:00:11]
- key: `DRIFT_BUCKET|drift ≥+30%: n=35 hit%=20.0% ROI=0.57 (コスト 9,000/回収 5,090)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-29T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=16 pred=0.0095 actual=0.0625 gap=-0.0530`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-29T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1957 actual=0.2000 gap=-0.0043`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-29T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=12 pred=0.2234 actual=0.4167 gap=-0.1933`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-29T06:00:11]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=38 hit%=28.9% ROI=1.03 (コスト 8,600/回収 8,840)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-05-29T06:00:11]
- key: `ROI_STAT|S00: n=176 hit%=28.4% hit_CI[Bonf]=[19.7,39.0]% ROI=0.96 ROI_boot95=[0.68,1.28]`
- **FIX**: 統計サマリ情報。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 3.77MB / last modified 2026-05-30T05:30:04.492065+09:00

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
74 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-29 23:55:06,974 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-29 23:55:07,019 [INFO] predictor: Models loaded OK
2026-05-29 23:55:07,023 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-29 23:56:06,353 [INFO] run_cycle: === run_cycle 23:56:06 ===
2026-05-29 23:56:06,353 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-29 23:56:06,353 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-29 23:56:06,422 [INFO] predictor: Models loaded OK
2026-05-29 23:56:06,426 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-29 23:57:06,452 [INFO] run_cycle: === run_cycle 23:57:06 ===
2026-05-29 23:57:06,452 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-29 23:57:06,452 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-29 23:57:06,496 [INFO] predictor: Models loaded OK
2026-05-29 23:57:06,500 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-29 23:58:06,469 [INFO] run_cycle: === run_cycle 23:58:06 ===
2026-05-29 23:58:06,470 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-29 23:58:06,470 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-29 23:58:06,544 [INFO] predictor: Models loaded OK
2026-05-29 23:58:06,554 [INFO] run_cycle: run_cycle done: 0 notifications
2026-05-29 23:59:05,932 [INFO] run_cycle: === run_cycle 23:59:05 ===
2026-05-29 23:59:05,932 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-05-29 23:59:05,932 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-29 23:59:05,977 [INFO] predictor: Models loaded OK
2026-05-29 23:59:05,981 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 65
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 65
  }
]
```

## Phase別通知記録 (24h)
{'final': 27, 'result': 15, 'scan': 23}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 101
  FINAL_MISSING: 52
  KS_ODDS_DRIFT: 42
  CIRCUIT_BREAKER_TRIP: 40
  CIRCUIT_BREAKER_NO_ACTION: 28
  PSI_DRIFT_DETECTED: 28
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 8
  ANOMALY_SCAN_FINAL_RATIO: 7
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 30 | 4 | 9,000 | 3,780 | -5,220 | 0.42 |
| S01_NAKAANA1 | 35 | 9 | 7,000 | 4,640 | -2,360 | 0.663 |
| S02_TETSUBAN | 11 | 7 | 2,200 | 2,880 | +680 | 1.309 |

## 直近アラート (24h・新しい順)
```
[23:49:05] FINAL_MISSING: {"deadline": "2026-05-29T12:11:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052908041211", "sid": "S01_NAKAANA1"}
[23:36:05] FINAL_MISSING: {"deadline": "2026-05-29T14:01:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052909081401", "sid": "S00"}
[23:28:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[23:26:06] FINAL_MISSING: {"deadline": "2026-05-29T10:47:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052902011047", "sid": "S00"}
[23:25:06] CIRCUIT_BREAKER_TRIP: {"cost": 7000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 4640, "roi_7d": 0.663, "sid": "S01_NAKAANA1"}
[23:25:06] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.007496, "ks_stat": 0.215}
[23:13:06] CIRCUIT_BREAKER_TRIP: {"cost": 9000, "kind": "CIRCUIT_BREAKER_TRIP", "n": 30, "payout": 3780, "roi_7d": 0.42, "sid": "S00"}
[23:09:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:09:05] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[22:59:06] FINAL_MISSING: {"deadline": "2026-05-29T12:20:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052923091220", "sid": "S00"}
```

## 本日残レース: 0件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 0件 登録 / 0件 締切済
- 通知発射: scan=0 nid / final=0 nid / result=0 nid
- predictions: 0 / うち結果DB記録済: 0
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 074R | win | 1 | 0.4480 | 3.7 | 1.66 | 200 | scan=- drift=- | 17:15:46 |
| S01_NAKAANA1 | 073R | win | 1 | 0.5123 | 4.4 | 2.25 | 200 | scan=- drift=- | 16:45:22 |
| S00 | 152R | win | 1 | 0.1034 | 4.0 | 0.41 | 300 | scan=- drift=- | 15:47:33 |
| S01_NAKAANA1 | 029R | win | 1 | 0.5123 | 3.0 | 1.54 | 200 | scan=- drift=- | 14:45:32 |
| S01_NAKAANA1 | 096R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=4.0 drift=-22.5% | 12:55:21 |
| S00 | 238R | win | 1 | 0.3177 | 27.7 | 8.80 | 300 | scan=- drift=- | 11:45:32 |
| S00 | 147R | win | 1 | 0.5735 | 6.3 | 3.61 | 300 | scan=13.0 drift=-51.5% | 11:29:21 |
| S00 | 093R | win | 1 | 0.5109 | 10.1 | 5.16 | 300 | scan=4.1 drift=+146.3% | 11:26:19 |
| S01_NAKAANA1 | 237R | win | 1 | 0.5123 | 3.3 | 1.69 | 200 | scan=4.5 drift=-26.7% | 11:18:34 |
| S00 | 146R | win | 1 | 0.5174 | 6.7 | 3.47 | 300 | scan=5.2 drift=+28.8% | 11:00:25 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 40 | -0.2% | -81.4% | +157.5% | 15 | 8 | 28 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 474.8s |
| **Latency** (scan→final max) | 622.7s |
| **Traffic** (notifications 24h) | 65 |
| **Errors** (send fail rate) | ✅ 0.0% |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 328 | 0.4553 | 0.3171 | +0.1383 | 🟡+30% | 0.2346 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 177 | 0.4225 | 0.2768 | 0.2230 | 🔴-0.11 | 0.941 |
| S01_NAKAANA1 | win | 100 | 0.4851 | 0.3000 | 0.2446 | 🔴-0.16 | 0.784 |
| S02_TETSUBAN | win | 51 | 0.5110 | 0.4902 | 0.2555 | 🔴-0.02 | 0.933 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 16 | 0.0095 | 0.0625 | 🔴-0.0530 |
| 0.10-0.15 | 5 | 0.1221 | 0.0000 | 🔴+0.1221 |
| 0.15-0.20 | 5 | 0.1957 | 0.2000 | ✅-0.0043 |
| 0.20-0.30 | 11 | 0.2239 | 0.4545 | 🔴-0.2306 |
| 0.30-0.50 | 141 | 0.4160 | 0.2766 | 🔴+0.1394 |
| 0.50+ | 160 | 0.5398 | 0.3688 | 🔴+0.1710 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 25 | 0.783 |
| win | <5.0 | ✅learned | 46 | 0.795 |
| win | <10.0 | ✅learned | 37 | 0.538 |
| win | <20.0 | ✅learned | 11 | 0.193 |
| win | <50.0 | ⚠️fallback | 1 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-05-30T05:50:01.849361+09:00_